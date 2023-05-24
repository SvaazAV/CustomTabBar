# Description

This code includes the implementation of a custom tab bar in SwiftUI. It provides a visual interface for switching between different tabs and displays corresponding content based on the selected tab.

# Code Overview

The code consists of two main components:

**1. CustomTabBar**

The CustomTabBar struct defines a custom tab bar view. It takes an array of TabInfo objects and a binding to the selected tab index as input. The tab bar is implemented using SwiftUI's ZStack and HStack views. Each tab is represented by a button with an image and a corresponding action that updates the selected tab index.  The appearance of the tab items can be customized by modifying the code.

**2. ContentView**

The ContentView struct represents the main view of the application. It includes the implementation of the tab bar and the content views for each tab. The selected tab index is managed using the @State property wrapper. Depending on the selected tab index, a different content view is displayed. In the provided code, four different content views (PurpleView, PinkView, GreenView, and BlueView) are used as examples.

# Usage

Customizing Content View

The tabs array in the ContentView struct allows you to define the tabs you want to display in the tab bar. You can add or remove items from this array based on your requirements. Each item in the array should be an instance of the TabInfo struct, representing a tab with a title and an image.

    struct ContentView: View {
        @State private var selectedTabIndex = 1

        let tabs: [TabInfo] = [
            // Add or remove items as needed
            TabInfo(title: "Search", image: "magnifyingglass"),
            TabInfo(title: "Home", image: "house.lodge"),
            TabInfo(title: "Collection", image: "books.vertical"),
            TabInfo(title: "Settings", image: "gearshape.fill")
        ]

        var body: some View {
            ZStack {
                switch selectedTabIndex {
                case 0:
                    // Display the content for the first tab
                    // Replace with your own content view
                case 1:
                    // Display the content for the second tab
                    // Replace with your own content view
                case 2:
                    // Display the content for the third tab
                    // Replace with your own content view
                default:
                    // Display the content for the fourth tab
                    // Replace with your own content view
                }

                VStack {
                    Spacer()
                    CustomTabBar(tabs: tabs, selectedTab: $selectedTabIndex)
                }
            }
        }
    }

Customizing CustomTabBar

The CustomTabBar struct can be customized to fit your needs. You can modify the code to adjust the alignment of the tab items, add text alongside the icons, and extend the functionality of the tab bar. By adjusting the HStack alignment property, you can align the tab items as desired. Uncommenting the Text view code within the Button allows you to display the titles of the tab items. Additionally, you have the flexibility to extend the functionality by modifying the code within the struct. Feel free to experiment and adapt the tab bar to match your project's specific requirements.

    struct CustomTabBar: View {

        let tabs: [TabInfo]
        @Binding var selectedTab: Int

        var body: some View {
            ZStack {
                RoundedRectangle(cornerRadius: 30)
                    // Add modifiers to customize the rectangle.
                    .foregroundColor(.white)
                    .frame(height: 60)
                    .shadow(radius: 25, y: 10)
                    .padding(.horizontal)

                HStack (alignment: .bottom) {
                    ForEach(0..<tabs.count, id: \.self) { currentTab in
                        Button {
                            // Changes the selected tab with an animation
                            withAnimation(.easeIn(duration: 0.2)) {
                                selectedTab = currentTab
                            }
                        } label: {
                            VStack {
                                Image(systemName: tabs[currentTab].image)
                                    .resizable()
                                    .aspectRatio(contentMode: .fit)
                                    .frame(maxWidth: .infinity, maxHeight: selectedTab == currentTab ? 30 : 20)
                                    .foregroundColor(selectedTab == currentTab ? .orange : .black)

                                Text(tabs[currentTab].title)
                                    .font(selectedTab == currentTab ? .headline : .subheadline)
                                    .foregroundColor(selectedTab == currentTab ? .orange : .black)

                            }
                        }

                    }
                }
                .padding(.horizontal)
            }
        }
    }

    struct TabInfo {
        let title: String
        let image: String
    }
